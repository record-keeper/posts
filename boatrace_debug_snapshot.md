# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-10T15:30:02.313225+09:00

### 次に取るべきアクション
> RED最優先: CALIBRATION_DRIFT×31 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×33 (24h)
- 🔴 CALIBRATION_DRIFT×31 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×5  [2026-09-10T15:25:29]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🔴 CALIBRATION_DRIFT  ×26  [2026-09-10T15:04:54]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×78  [2026-09-10T15:04:54]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×78  [2026-09-10T15:04:54]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×26  [2026-09-10T15:04:54]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×33  [2026-09-10T14:04:23]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-10T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-10T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-09-10T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×28  [2026-09-10T10:37:49]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=182<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-09-10T06:00:16]
- key: `ORPHAN_SCAN|194 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-10T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=190<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-10T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=9 pred=0.1773 actual=0.2222 gap=-0.0449`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-09-10T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=46 pred=0.3225 actual=0.3043 gap=+0.0182`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S00: n=182 hit%=26.4% hit_CI[Bonf]=[18.1,36.7]% ROI=0.90 ROI_boot95=[0.64,1.19]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=190 hit%=23.7% hit_CI[Bonf]=[16.0,33.6]% ROI=0.74 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-10T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=35.7% hit_CI[Bonf]=[22.6,51.5]% ROI=0.63 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-10T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.63 (コスト 10,700/回収 6,700)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 12.84MB / last modified 2026-09-10T15:29:37.852040+09:00

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
 loaded OK
2026-09-10 15:28:05,648 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-10 15:29:05,628 [INFO] run_cycle: === run_cycle 15:29:05 ===
2026-09-10 15:29:05,628 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 15:29:05,628 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 15:29:05,675 [INFO] predictor: Models loaded OK
2026-09-10 15:29:17,080 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=2&jcd=01&hd=20260910: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-09-10 15:29:28,474 [INFO] scraper: odds3t: 120/120 parsed
2026-09-10 15:29:29,579 [INFO] scraper: odds3f: 20/20 parsed
2026-09-10 15:29:30,678 [INFO] scraper: odds2t: 30/30 parsed
2026-09-10 15:29:30,679 [INFO] scraper: odds2f: 15/15 parsed
2026-09-10 15:29:31,866 [INFO] scraper: odds_win: 4/6 parsed
2026-09-10 15:29:31,866 [INFO] scraper: fetch_race 01/2: boats=6 odds=189/191
2026-09-10 15:29:31,870 [INFO] predictor: CALIBRATION_MODE=on
2026-09-10 15:29:31,870 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-09-10 15:29:31,874 [INFO] run_cycle: fetched 01/2 [scan]: 154 combos
2026-09-10 15:29:35,342 [INFO] race_id: notif: nid=2026091001021542 sid=S01_NAKAANA1 phase=scan rank=B
2026-09-10 15:29:35,896 [INFO] notifier: Discord notify OK (status=204)
2026-09-10 15:29:37,046 [INFO] notifier: Discord notify OK (status=204)
2026-09-10 15:29:37,456 [INFO] run_cycle: SCAN S01_NAKAANA1 桐生2R B
2026-09-10 15:29:37,651 [INFO] run_cycle: run_cycle done: 1 notifications
2026-09-10 15:30:08,212 [INFO] run_cycle: === run_cycle 15:30:08 ===
2026-09-10 15:30:08,213 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-10 15:30:08,213 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-10 15:30:08,310 [INFO] predictor: Models loaded OK

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
{'final': 32, 'result': 15, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 146
  FINAL_MISSING: 33
  CALIBRATION_DRIFT: 31
  CIRCUIT_BREAKER_TRIP: 31
  CIRCUIT_BREAKER_NO_ACTION: 23
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 6
  ANOMALY_BET_VOLUME_SPIKE: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 33 | 5 | 9,900 | 4,890 | -5,010 | 0.494 |
| S01_NAKAANA1 | 45 | 9 | 9,000 | 5,620 | -3,380 | 0.624 |
| S02_TETSUBAN | 22 | 7 | 4,400 | 2,180 | -2,220 | 0.495 |

## 直近アラート (24h・新しい順)
```
[15:27:35] FINAL_MISSING: {"deadline": "2026-09-10T10:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091004011055", "sid": "S00"}
[15:25:28] CIRCUIT_BREAKER_TRIP: {"cost": 9000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 45, "payout": 5620, "roi_7d": 0.624, "sid": "S01_NAKAANA1"}
[15:25:28] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 10.6, "baseline_n_days": 7, "baseline_stdev": 2.1, "hour": 15, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 15, "z_score": 2.06}
[15:24:27] FINAL_MISSING: {"deadline": "2026-09-10T13:53:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091004071353", "sid": "S00"}
[15:13:53] FINAL_MISSING: {"deadline": "2026-09-10T11:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091003021141", "sid": "S00"}
[15:11:26] FINAL_MISSING: {"deadline": "2026-09-10T10:38:00+09:00", "kind": "FINAL_MISSING", "nid": "2026091013011038", "sid": "S00"}
[15:07:43] CIRCUIT_BREAKER_TRIP: {"cost": 4400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 22, "payout": 2180, "roi_7d": 0.495, "sid": "S02_TETSUBAN"}
[15:06:06] CIRCUIT_BREAKER_TRIP: {"cost": 9900, "kind": "CIRCUIT_BREAKER_TRIP", "n": 33, "payout": 4890, "roi_7d": 0.494, "sid": "S00"}
[15:04:52] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:04:52] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
```

## 本日残レース: 46件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 132件 登録 / 86件 締切済
- 通知発射: scan=22 nid / final=24 nid / result=13 nid
- predictions: 15 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 6件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 1610R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 15:25:20 |
| S02_TETSUBAN | 1310R | win | 1 | 0.4111 | 2.3 | 0.95 | 200 | scan=- drift=- | 15:07:27 |
| S00 | 178R | win | 1 | 0.5891 | 7.0 | 4.12 | 300 | scan=6.2 drift=+12.9% | 14:07:21 |
| S02_TETSUBAN | 036R | win | 1 | 0.5123 | 2.4 | 1.23 | 200 | scan=2.4 drift=+0.0% | 13:26:20 |
| S00 | 045R | win | 1 | 0.4989 | 10.5 | 5.24 | 300 | scan=7.1 drift=+47.9% | 12:49:20 |
| S02_TETSUBAN | 034R | win | 1 | 0.4111 | 2.0 | 0.82 | 200 | scan=- drift=- | 12:32:22 |
| S00 | 054R | win | 1 | 0.2082 | 4.4 | 0.92 | 300 | scan=- drift=- | 12:28:23 |
| S01_NAKAANA1 | 053R | win | 1 | 0.5073 | 3.0 | 1.52 | 200 | scan=4.5 drift=-33.3% | 11:58:26 |
| S01_NAKAANA1 | 043R | win | 1 | 0.4111 | 4.8 | 1.97 | 200 | scan=- drift=- | 11:50:34 |
| S02_TETSUBAN | 032R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=- drift=- | 11:39:21 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 59 | +6.2% | -75.5% | +137.8% | 19 | 9 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 435.1s |
| **Latency** (scan→final max) | 600.3s |
| **Traffic** (notifications 24h) | 77 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |
| **Saturation** (S02_TETSUBAN) | 1,000円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 457 | 0.4715 | 0.2691 | +0.2023 | 🟡+43% | 0.2402 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 183 | 0.4238 | 0.2568 | 0.2184 | 🔴-0.14 | 0.88 |
| S01_NAKAANA1 | win | 187 | 0.4843 | 0.2406 | 0.2490 | 🔴-0.36 | 0.748 |
| S02_TETSUBAN | win | 87 | 0.5441 | 0.3563 | 0.2673 | 🔴-0.17 | 0.622 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1314 | 0.0000 | 🔴+0.1314 |
| 0.15-0.20 | 9 | 0.1773 | 0.2222 | ✅-0.0449 |
| 0.20-0.30 | 8 | 0.2235 | 0.1250 | 🔴+0.0985 |
| 0.30-0.50 | 165 | 0.4033 | 0.2242 | 🔴+0.1791 |
| 0.50+ | 265 | 0.5451 | 0.3094 | 🔴+0.2356 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 134 | 0.771 |
| win | <5.0 | ✅learned | 242 | 0.748 |
| win | <10.0 | ✅learned | 118 | 0.471 |
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
_auto-generated by claude_snapshot.py at 2026-09-10T15:30:02.313225+09:00_