# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-15T18:30:02.192063+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×45 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×83 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×45 (24h)
- 🔴 PSI_DRIFT_DETECTED×19 (24h)
- 🔴 CALIBRATION_DRIFT×18 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-15T18:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-15T18:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×50  [2026-09-15T18:05:21]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×50  [2026-09-15T18:05:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×25  [2026-09-15T18:05:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 PSI_DRIFT_DETECTED  ×30  [2026-09-15T18:00:13]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 CALIBRATION_DRIFT  ×52  [2026-09-15T17:38:37]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×10  [2026-09-15T13:44:26]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×9  [2026-09-15T12:53:05]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-15T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S00: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-15T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=82<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-15T06:00:05]
- key: `ORPHAN_SCAN|172 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-15T06:00:05]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=179<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-15T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1314 actual=0.0000 gap=+0.1314`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-15T06:00:05]
- key: `DRIFT_BUCKET|drift ≤-30%: n=33 hit%=24.2% ROI=0.69 (コスト 9,500/回収 6,560)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-15T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=6 pred=0.1783 actual=0.3333 gap=-0.1550`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-15T06:00:05]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=40 pred=0.3232 actual=0.3000 gap=+0.0232`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-15T06:00:05]
- key: `ROI_STAT|S00: n=167 hit%=26.9% hit_CI[Bonf]=[18.3,37.8]% ROI=0.93 ROI_boot95=[0.63,1.26]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-15T06:00:05]
- key: `ROI_STAT|S01_NAKAANA1: n=179 hit%=25.1% hit_CI[Bonf]=[17.0,35.5]% ROI=0.75 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-15T06:00:05]
- key: `ROI_STAT|S02_TETSUBAN: n=82 hit%=35.4% hit_CI[Bonf]=[22.1,51.3]% ROI=0.62 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 13.31MB / last modified 2026-09-15T18:30:05.286850+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
26-09-15 18:29:04,608 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-15 18:29:04,675 [INFO] predictor: Models loaded OK
2026-09-15 18:29:15,745 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=8&jcd=07&hd=20260915: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-15 18:29:27,221 [INFO] scraper: odds3t: 120/120 parsed
2026-09-15 18:29:28,366 [INFO] scraper: odds3f: 20/20 parsed
2026-09-15 18:29:29,467 [INFO] scraper: odds2t: 29/30 parsed
2026-09-15 18:29:29,468 [INFO] scraper: odds2f: 15/15 parsed
2026-09-15 18:29:30,552 [INFO] scraper: odds_win: 6/6 parsed
2026-09-15 18:29:30,552 [INFO] scraper: fetch_race 07/8: boats=6 odds=190/191
2026-09-15 18:29:30,555 [INFO] predictor: CALIBRATION_MODE=on
2026-09-15 18:29:30,555 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-09-15 18:29:30,559 [INFO] run_cycle: fetched 07/8 [final]: 155 combos
2026-09-15 18:29:31,207 [INFO] race_id: notif: nid=2026091507081832 sid=S02_TETSUBAN phase=final rank=
2026-09-15 18:29:31,546 [INFO] notifier: Discord notify OK (status=204)
2026-09-15 18:29:32,456 [INFO] notifier: Discord notify OK (status=204)
2026-09-15 18:29:32,489 [INFO] run_cycle: RETREAT S02_TETSUBAN 蒲郡8R
2026-09-15 18:29:35,919 [INFO] scraper: odds3t: 120/120 parsed
2026-09-15 18:29:36,998 [INFO] scraper: odds3f: 20/20 parsed
2026-09-15 18:29:38,081 [INFO] scraper: odds2t: 30/30 parsed
2026-09-15 18:29:38,082 [INFO] scraper: odds2f: 15/15 parsed
2026-09-15 18:29:39,186 [INFO] scraper: odds_win: 6/6 parsed
2026-09-15 18:29:39,186 [INFO] scraper: fetch_race 20/8: boats=6 odds=191/191
2026-09-15 18:29:39,189 [INFO] predictor: CALIBRATION_MODE=on
2026-09-15 18:29:39,189 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-15 18:29:39,193 [INFO] run_cycle: fetched 20/8 [scan]: 156 combos
2026-09-15 18:29:39,299 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 77
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 77
  }
]
```

## Phase別通知記録 (24h)
{'final': 31, 'result': 14, 'scan': 32}

## アラート件数 (24h・種類別)
```
  FINAL_MISSING: 83
  ANOMALY_SCRAPER_FAILURE_BURST: 48
  CIRCUIT_BREAKER_TRIP: 45
  CIRCUIT_BREAKER_NO_ACTION: 39
  PSI_DRIFT_DETECTED: 19
  CALIBRATION_DRIFT: 18
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 8
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 6 | 9,300 | 4,860 | -4,440 | 0.523 |
| S01_NAKAANA1 | 35 | 8 | 7,000 | 4,440 | -2,560 | 0.634 |
| S02_TETSUBAN | 17 | 6 | 3,400 | 1,680 | -1,720 | 0.494 |

## 直近アラート (24h・新しい順)
```
[18:29:39] FINAL_MISSING: {"deadline": "2026-09-15T12:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091511061255", "sid": "S00"}
[18:25:05] FINAL_MISSING: {"deadline": "2026-09-15T12:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091504051252", "sid": "S00"}
[18:06:05] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4440, "roi_7d": 0.634, "sid": "S01_NAKAANA1"}
[18:06:05] CIRCUIT_BREAKER_TRIP: {"cost": 9300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 31, "payout": 4860, "roi_7d": 0.523, "sid": "S00"}
[18:06:05] FINAL_MISSING: {"deadline": "2026-09-15T13:34:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091509071334", "sid": "S00"}
[18:05:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[18:05:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[18:05:20] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[17:55:33] FINAL_MISSING: {"deadline": "2026-09-15T12:22:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091504041222", "sid": "S00"}
[17:52:15] FINAL_MISSING: {"deadline": "2026-09-15T10:18:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091510051018", "sid": "S00"}
```

## 本日残レース: 19件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 137件 締切済
- 通知発射: scan=26 nid / final=24 nid / result=11 nid
- predictions: 12 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 075R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=4.2 drift=+4.8% | 17:05:45 |
| S00 | 075R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=4.2 drift=+4.8% | 17:05:32 |
| S00 | 124R | win | 1 | 0.5476 | 7.2 | 3.94 | 300 | scan=9.2 drift=-21.7% | 16:30:24 |
| S02_TETSUBAN | 203R | win | 1 | 0.5990 | 2.1 | 1.26 | 200 | scan=- drift=- | 16:13:31 |
| S00 | 1111R | win | 1 | 0.5891 | 4.7 | 2.77 | 300 | scan=5.2 drift=-9.6% | 15:30:39 |
| S01_NAKAANA1 | 088R | win | 1 | 0.5998 | 3.0 | 1.80 | 200 | scan=- drift=- | 14:04:19 |
| S00 | 118R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=5.6 drift=+33.9% | 13:54:31 |
| S01_NAKAANA1 | 148R | win | 1 | 0.5891 | 3.8 | 2.24 | 200 | scan=3.5 drift=+8.6% | 12:02:18 |
| S00 | 114R | win | 1 | 0.4111 | 4.3 | 1.77 | 300 | scan=21.7 drift=-80.2% | 11:54:30 |
| S00 | 093R | win | 1 | 0.5174 | 4.0 | 2.07 | 300 | scan=- drift=- | 11:31:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 50 | +5.2% | -80.2% | +93.9% | 12 | 3 | 30 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 520.9s |
| **Latency** (scan→final max) | 613.6s |
| **Traffic** (notifications 24h) | 77 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 2,400円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 427 | 0.4755 | 0.2740 | +0.2015 | 🟡+42% | 0.2419 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 173 | 0.4349 | 0.2717 | 0.2256 | 🔴-0.14 | 0.941 |
| S01_NAKAANA1 | win | 174 | 0.4836 | 0.2471 | 0.2469 | 🔴-0.33 | 0.759 |
| S02_TETSUBAN | win | 80 | 0.5458 | 0.3375 | 0.2665 | 🔴-0.19 | 0.603 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 6 | 0.1783 | 0.3333 | 🔴-0.1550 |
| 0.20-0.30 | 7 | 0.2214 | 0.0000 | 🔴+0.2214 |
| 0.30-0.50 | 154 | 0.4041 | 0.2338 | 🔴+0.1704 |
| 0.50+ | 251 | 0.5465 | 0.3108 | 🔴+0.2357 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 138 | 0.766 |
| win | <5.0 | ✅learned | 250 | 0.753 |
| win | <10.0 | ✅learned | 122 | 0.466 |
| win | <20.0 | ✅learned | 31 | 0.231 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-09-15T18:30:02.192063+09:00_