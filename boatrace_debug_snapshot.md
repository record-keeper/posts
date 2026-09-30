# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-09-30T13:40:02.171125+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×40 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×98 (24h)
- 🔴 PSI_DRIFT_DETECTED×40 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×34 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-30T13:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-09-30T13:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×68  [2026-09-30T13:06:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×68  [2026-09-30T13:06:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×34  [2026-09-30T13:06:05]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×34  [2026-09-30T13:06:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×34  [2026-09-30T12:10:44]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_ODDS_SHIFT  ×57  [2026-09-30T11:51:36]
- key: `ANOMALY_ODDS_SHIFT|`
- **FIX**: odds 分布が2σシフト。scraper format変化・市場変動・戦略filterレンジ変更

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×8  [2026-09-30T11:46:40]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×51  [2026-09-30T11:00:49]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### 🟡 ORPHAN_SCAN  ×1  [2026-09-30T06:00:36]
- key: `ORPHAN_SCAN|175 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-30T06:00:36]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=78<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-30T06:00:36]
- key: `INSUFFICIENT_SAMPLE|S00: n=164<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-09-30T06:00:36]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-09-30T06:00:36]
- key: `ROI_STAT|S00: n=164 hit%=21.3% hit_CI[Bonf]=[13.6,31.8]% ROI=0.64 ROI_boot95=[0.41,0.89]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-30T06:00:36]
- key: `ROI_STAT|S01_NAKAANA1: n=165 hit%=23.0% hit_CI[Bonf]=[15.0,33.6]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-09-30T06:00:36]
- key: `ROI_STAT|S02_TETSUBAN: n=78 hit%=47.4% hit_CI[Bonf]=[32.2,63.2]% ROI=0.81 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift ≤-30%: n=28 hit%=35.7% ROI=1.04 (コスト 7,800/回収 8,130)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=44 hit%=25.0% ROI=0.67 (コスト 10,200/回収 6,790)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-09-30T06:00:36]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=23.9% ROI=0.69 (コスト 21,400/回収 14,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 14.56MB / last modified 2026-09-30T13:39:21.728287+09:00

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
=== run_cycle 13:38:04 ===
2026-09-30 13:38:04,583 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-30 13:38:04,583 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-30 13:38:04,634 [INFO] predictor: Models loaded OK
2026-09-30 13:38:16,385 [INFO] scraper: odds3t: 120/120 parsed
2026-09-30 13:38:17,460 [INFO] scraper: odds3f: 20/20 parsed
2026-09-30 13:38:18,555 [INFO] scraper: odds2t: 30/30 parsed
2026-09-30 13:38:18,556 [INFO] scraper: odds2f: 14/15 parsed
2026-09-30 13:38:19,642 [INFO] scraper: odds_win: 6/6 parsed
2026-09-30 13:38:19,642 [INFO] scraper: fetch_race 02/7: boats=6 odds=190/191
2026-09-30 13:38:19,646 [INFO] predictor: CALIBRATION_MODE=on
2026-09-30 13:38:19,646 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-09-30 13:38:19,650 [INFO] run_cycle: fetched 02/7 [scan]: 156 combos
2026-09-30 13:38:19,985 [INFO] run_cycle: run_cycle done: 0 notifications
2026-09-30 13:39:04,818 [INFO] run_cycle: === run_cycle 13:39:04 ===
2026-09-30 13:39:04,818 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-09-30 13:39:04,818 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-09-30 13:39:04,891 [INFO] predictor: Models loaded OK
2026-09-30 13:39:17,411 [INFO] scraper: odds3t: 120/120 parsed
2026-09-30 13:39:18,485 [INFO] scraper: odds3f: 20/20 parsed
2026-09-30 13:39:19,618 [INFO] scraper: odds2t: 30/30 parsed
2026-09-30 13:39:19,619 [INFO] scraper: odds2f: 15/15 parsed
2026-09-30 13:39:20,689 [INFO] scraper: odds_win: 5/6 parsed
2026-09-30 13:39:20,690 [INFO] scraper: fetch_race 06/6: boats=6 odds=190/191
2026-09-30 13:39:20,693 [INFO] predictor: CALIBRATION_MODE=on
2026-09-30 13:39:20,693 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-09-30 13:39:20,697 [INFO] run_cycle: fetched 06/6 [scan]: 155 combos
2026-09-30 13:39:20,885 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 63
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 63
  }
]
```

## Phase別通知記録 (24h)
{'final': 23, 'result': 14, 'scan': 26}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 138
  FINAL_MISSING: 98
  PSI_DRIFT_DETECTED: 40
  CIRCUIT_BREAKER_NO_ACTION: 34
  CIRCUIT_BREAKER_TRIP: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 7
  ANOMALY_SCAN_FINAL_RATIO: 4
  ANOMALY_ODDS_SHIFT: 2
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 6 | 11,100 | 4,440 | -6,660 | 0.4 |
| S01_NAKAANA1 | 41 | 11 | 8,200 | 5,360 | -2,840 | 0.654 |
| S02_TETSUBAN | 25 | 14 | 5,000 | 4,900 | -100 | 0.98 |

## 直近アラート (24h・新しい順)
```
[13:24:40] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 4440, "roi_7d": 0.4, "sid": "S00"}
[13:24:40] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 307, "n_recent": 103, "psi": 0.374}
[13:21:47] CIRCUIT_BREAKER_TRIP: {"cost": 8200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 5360, "roi_7d": 0.654, "sid": "S01_NAKAANA1"}
[13:21:47] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 306, "n_recent": 103, "psi": 0.374}
[13:20:49] FINAL_MISSING: {"deadline": "2026-09-30T09:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026093014040950", "sid": "S00"}
[13:11:28] FINAL_MISSING: {"deadline": "2026-09-30T12:41:00+09:00", "kind": "FINAL_MISSING", "nid": "2026093023091241", "sid": "S00"}
[13:03:31] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[13:03:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[13:03:31] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[13:02:33] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 305, "n_recent": 103, "psi": 0.377}
```

## 本日残レース: 81件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 63件 締切済
- 通知発射: scan=15 nid / final=15 nid / result=6 nid
- predictions: 8 / うち結果DB記録済: 6
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 166R | win | 1 | 0.5123 | 2.7 | 1.38 | 200 | scan=- drift=- | 13:24:20 |
| S01_NAKAANA1 | 097R | win | 1 | 0.4111 | 3.0 | 1.23 | 200 | scan=- drift=- | 13:21:21 |
| S00 | 055R | win | 1 | 0.5208 | 6.3 | 3.28 | 300 | scan=- drift=- | 13:02:20 |
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 3.6 | 1.48 | 200 | scan=3.0 drift=+20.0% | 12:51:32 |
| S00 | 149R | win | 1 | 0.4111 | 11.4 | 4.69 | 300 | scan=48.0 drift=-76.2% | 12:24:21 |
| S00 | 043R | win | 1 | 0.5123 | 34.5 | 17.67 | 300 | scan=- drift=- | 11:51:20 |
| S00 | 041R | win | 1 | 0.3177 | 6.5 | 2.07 | 300 | scan=20.2 drift=-67.8% | 10:53:20 |
| S01_NAKAANA1 | 145R | win | 1 | 0.4978 | 3.9 | 1.94 | 200 | scan=4.0 drift=-2.5% | 10:13:31 |
| S02_TETSUBAN | 078R | win | 1 | 0.5334 | 2.2 | 1.17 | 200 | scan=2.0 drift=+10.0% | 18:38:32 |
| S02_TETSUBAN | 074R | win | 1 | 0.5891 | 2.1 | 1.24 | 200 | scan=- drift=- | 16:39:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +7.3% | -76.2% | +357.1% | 20 | 7 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 501.1s |
| **Latency** (scan→final max) | 606.1s |
| **Traffic** (notifications 24h) | 63 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 408 | 0.4795 | 0.2721 | +0.2075 | 🟡+43% | 0.2455 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 166 | 0.4503 | 0.2169 | 0.2397 | 🔴-0.41 | 0.654 |
| S01_NAKAANA1 | win | 165 | 0.4880 | 0.2303 | 0.2472 | 🔴-0.39 | 0.676 |
| S02_TETSUBAN | win | 77 | 0.5243 | 0.4805 | 0.2543 | 🔴-0.02 | 0.819 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.30-0.50 | 155 | 0.4143 | 0.2323 | 🔴+0.1820 |
| 0.50+ | 238 | 0.5439 | 0.3025 | 🔴+0.2414 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 163 | 0.771 |
| win | <5.0 | ✅learned | 277 | 0.752 |
| win | <10.0 | ✅learned | 127 | 0.462 |
| win | <20.0 | ✅learned | 34 | 0.237 |
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
_auto-generated by claude_snapshot.py at 2026-09-30T13:40:02.171125+09:00_