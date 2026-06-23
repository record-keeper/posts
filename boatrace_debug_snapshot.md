# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-23T14:20:02.064764+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×42 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×46 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×42 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CALIBRATION_DRIFT×2 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×30  [2026-06-23T14:05:39]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×30  [2026-06-23T14:05:39]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×15  [2026-06-23T14:05:39]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-23T13:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-06-23T13:30:05]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×26  [2026-06-23T11:39:06]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×22  [2026-06-23T11:28:21]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×4  [2026-06-23T11:01:21]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×21  [2026-06-23T09:37:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-23T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S00: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-23T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.1111 gap=+0.1130`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-23T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.05-0.10: n=5 pred=0.0816 actual=0.0000 gap=+0.0816`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-23T06:00:17]
- key: `DRIFT_BUCKET|drift ≤-30%: n=34 hit%=20.6% ROI=0.67 (コスト 9,700/回収 6,510)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-23T06:00:17]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1808 actual=0.4286 gap=-0.2478`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-23T06:00:17]
- key: `ROI_STAT|S00: n=153 hit%=24.8% hit_CI[Bonf]=[16.2,36.0]% ROI=0.67 ROI_boot95=[0.47,0.88]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-23T06:00:17]
- key: `ROI_STAT|S01_NAKAANA1: n=139 hit%=27.3% hit_CI[Bonf]=[17.9,39.3]% ROI=0.73 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-23T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=139<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-23T06:00:17]
- key: `ROI_STAT|S02_TETSUBAN: n=76 hit%=34.2% hit_CI[Bonf]=[20.8,50.8]% ROI=0.58 ROI_boot95=[0.3`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-23T06:00:17]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=76<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-23T06:00:17]
- key: `ORPHAN_SCAN|157 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 5.75MB / last modified 2026-06-23T14:19:22.012054+09:00

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
t=5000
2026-06-23 14:18:06,037 [INFO] predictor: Models loaded OK
2026-06-23 14:18:17,303 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=9&jcd=11&hd=20260623: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-23 14:18:28,837 [INFO] scraper: odds3t: 120/120 parsed
2026-06-23 14:18:29,946 [INFO] scraper: odds3f: 20/20 parsed
2026-06-23 14:18:31,046 [INFO] scraper: odds2t: 27/30 parsed
2026-06-23 14:18:31,047 [INFO] scraper: odds2f: 14/15 parsed
2026-06-23 14:18:32,177 [INFO] scraper: odds_win: 2/6 parsed
2026-06-23 14:18:32,177 [INFO] scraper: fetch_race 11/9: boats=6 odds=183/191
2026-06-23 14:18:32,189 [INFO] predictor: CALIBRATION_MODE=on
2026-06-23 14:18:32,189 [INFO] predictor: combos: {'win': 2, '2t': 27, '3t': 120}
2026-06-23 14:18:32,196 [INFO] run_cycle: fetched 11/9 [scan]: 149 combos
2026-06-23 14:18:32,348 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-23 14:19:05,529 [INFO] run_cycle: === run_cycle 14:19:05 ===
2026-06-23 14:19:05,530 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-23 14:19:05,530 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-23 14:19:05,574 [INFO] predictor: Models loaded OK
2026-06-23 14:19:18,166 [INFO] scraper: odds3t: 120/120 parsed
2026-06-23 14:19:19,318 [INFO] scraper: odds3f: 20/20 parsed
2026-06-23 14:19:20,520 [INFO] scraper: odds2t: 28/30 parsed
2026-06-23 14:19:20,521 [INFO] scraper: odds2f: 13/15 parsed
2026-06-23 14:19:21,677 [INFO] scraper: odds_win: 5/6 parsed
2026-06-23 14:19:21,677 [INFO] scraper: fetch_race 08/9: boats=6 odds=186/191
2026-06-23 14:19:21,688 [INFO] predictor: CALIBRATION_MODE=on
2026-06-23 14:19:21,689 [INFO] predictor: combos: {'win': 5, '2t': 28, '3t': 120}
2026-06-23 14:19:21,695 [INFO] run_cycle: fetched 08/9 [scan]: 153 combos
2026-06-23 14:19:21,910 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 62
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 62
  }
]
```

## Phase別通知記録 (24h)
{'final': 25, 'result': 10, 'scan': 27}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 81
  FINAL_MISSING: 46
  CIRCUIT_BREAKER_TRIP: 42
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_BET_VOLUME_DROP: 2
  CALIBRATION_DRIFT: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 11 | 12,300 | 8,580 | -3,720 | 0.698 |
| S01_NAKAANA1 | 37 | 8 | 7,400 | 3,820 | -3,580 | 0.516 |
| S02_TETSUBAN | 13 | 4 | 2,600 | 1,460 | -1,140 | 0.562 |

## 直近アラート (24h・新しい順)
```
[14:17:08] FINAL_MISSING: {"deadline": "2026-06-23T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062302031145", "sid": "S00"}
[14:12:05] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 8580, "roi_7d": 0.698, "sid": "S00"}
[14:04:21] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[14:04:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:04:21] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:47:29] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 3820, "roi_7d": 0.516, "sid": "S01_NAKAANA1"}
[13:34:40] CIRCUIT_BREAKER_TRIP: {"cost": 12900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 43, "payout": 8580, "roi_7d": 0.665, "sid": "S00"}
[13:27:34] CIRCUIT_BREAKER_TRIP: {"cost": 7200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 36, "payout": 3820, "roi_7d": 0.531, "sid": "S01_NAKAANA1"}
[13:23:46] CIRCUIT_BREAKER_TRIP: {"cost": 12600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 42, "payout": 8580, "roi_7d": 0.681, "sid": "S00"}
[13:16:30] FINAL_MISSING: {"deadline": "2026-06-23T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026062302031145", "sid": "S00"}
```

## 本日残レース: 71件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 73件 締切済
- 通知発射: scan=15 nid / final=15 nid / result=6 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 066R | win | 1 | 0.5063 | 4.5 | 2.28 | 200 | scan=- drift=- | 13:47:21 |
| S00 | 223R | win | 1 | 0.2290 | 7.1 | 1.63 | 300 | scan=7.1 drift=+0.0% | 13:34:32 |
| S00 | 166R | win | 1 | 0.1760 | 25.5 | 4.49 | 300 | scan=6.0 drift=+325.0% | 13:23:31 |
| S00 | 116R | win | 1 | 0.4989 | 16.5 | 8.23 | 300 | scan=- drift=- | 12:53:44 |
| S01_NAKAANA1 | 238R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=4.8 drift=-27.1% | 11:56:25 |
| S01_NAKAANA1 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=- drift=- | 11:34:23 |
| S00 | 083R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=- drift=- | 11:34:21 |
| S00 | 082R | win | 1 | 0.4111 | 5.2 | 2.14 | 300 | scan=- drift=- | 11:05:32 |
| S00 | 156R | win | 1 | 0.4111 | 7.2 | 2.96 | 300 | scan=9.7 drift=-25.8% | 17:35:23 |
| S00 | 193R | win | 1 | 0.5891 | 12.3 | 7.25 | 300 | scan=4.1 drift=+200.0% | 16:20:35 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +16.9% | -61.4% | +482.2% | 18 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 496.5s |
| **Latency** (scan→final max) | 611.7s |
| **Traffic** (notifications 24h) | 62 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 366 | 0.4728 | 0.2869 | +0.1859 | 🟡+39% | 0.2410 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 154 | 0.4248 | 0.2532 | 0.2231 | 🔴-0.18 | 0.678 |
| S01_NAKAANA1 | win | 136 | 0.4898 | 0.2941 | 0.2457 | 🔴-0.18 | 0.779 |
| S02_TETSUBAN | win | 76 | 0.5397 | 0.3421 | 0.2689 | 🔴-0.19 | 0.582 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.05-0.10 | 5 | 0.0816 | 0.0000 | 🔴+0.0816 |
| 0.15-0.20 | 8 | 0.1802 | 0.3750 | 🔴-0.1948 |
| 0.20-0.30 | 10 | 0.2246 | 0.1000 | 🔴+0.1246 |
| 0.30-0.50 | 123 | 0.4217 | 0.2439 | 🔴+0.1778 |
| 0.50+ | 215 | 0.5426 | 0.3256 | 🔴+0.2170 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 46 | 0.733 |
| win | <5.0 | ✅learned | 91 | 0.731 |
| win | <10.0 | ✅learned | 56 | 0.499 |
| win | <20.0 | ✅learned | 15 | 0.207 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-06-23T14:20:02.064764+09:00_